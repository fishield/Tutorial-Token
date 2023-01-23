
1. - GIT CLONE https://github.com/fishield/Tutorial-Token 

- INSTALL

"npm install @metaplex-foundation/mpl-token-metadata --save"
"npm install @solana/web3.js --save"
"npm install @project-serum/anchor --save"
"npm i ts-node --save"

Install solana https://docs.solana.com/cli/install-solana-cli-tools (pilih versi sesuai os)

=============================================================================

2. BUAT WALLET & TOKEN ADDRESS

- BUAT WALLET UTAMA

"solana-keygen new -o wallet-utama.json"

=============================================================================
output:
-----------------------------------------------------------------------------
Wrote new keypair to wallet-utama.json 
pubkey: 9LSj1J1LCJAuEAALJJiUk24JJZKEakBiwDtMnWnYRHYz 
-----------------------------------------------------------------------------
Save this seed phrase and your BIP39 passphrase to recover your new keypair:
region morning unknown manage pact cabin now fringe scrap hamster office whip
=============================================================================

- BUAT TOKEN ADDRESS

"solana-keygen grind --starts-with Kdo:1" (bebas mau Kdo atau apa juga)

=============================================================================
output:
-----------------------------------------------------------------------------
Searching with 4 threads for:
        1 pubkey that starts with 'Kdo' and ends with ''
Wrote keypair to kdoVcMtXDdzfDEDSyifG7sLMx6zzpZGD7Hwn5MjoiSs.json
=============================================================================

4. ADD RPC DEVNET 

"solana config set --url https://api.devnet.solana.com --keypair wallet-utama.json"

=============================================================================
output:
-----------------------------------------------------------------------------
Config File: C:\Users\Administrator\.config\solana\cli\config.yml
RPC URL: https://api.devnet.solana.com
WebSocket URL: wss://api.devnet.solana.com/ (computed)
Keypair Path: wallet-utama.json
Commitment: confirmed
=============================================================================

5. ADD BALANCE SOLANA (DEVNET) 

"solana airdrop 2"

=============================================================================
output:
-----------------------------------------------------------------------------
Requesting airdrop of 2 SOL
Signature: 3V74nC8zXfGuZvzLmymKxeRhxNqwqjzYAigFqHYf1RsAZDP5SoxZczERaYpuqJ3TjAJDZiyTH8y9DXastSVuKryh
=============================================================================

6. BUAT TOKEN 

"spl-token create-token kdoVcMtXDdzfDEDSyifG7sLMx6zzpZGD7Hwn5MjoiSs.json"

=============================================================================
output:
-----------------------------------------------------------------------------
Creating token kdoVcMtXDdzfDEDSyifG7sLMx6zzpZGD7Hwn5MjoiSs under program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA

Address:  kdoVcMtXDdzfDEDSyifG7sLMx6zzpZGD7Hwn5MjoiSs
Decimals:  9

Signature: 4AgawRhksendCpg75xyxPjwvXscFSGbcMG92LaQujWdQCWGnRjzmNM9gF5SppGFQ7nFCrY4nvHDdUfxUDT7H8ZrP
=============================================================================

7.  BUAT AKUN TOKEN

"spl-token create-account kdoVcMtXDdzfDEDSyifG7sLMx6zzpZGD7Hwn5MjoiSs"

=============================================================================
output:
-----------------------------------------------------------------------------
Creating account C1JX4BirMpnzZxKR2VjB4vnTAudqUsJkcnc9aLjpB6Nj

Signature: 2QiRAGqzrRpvQaUjE8uG8hbNWqeuN9v8NhTpbdhCzWoiE29pt8Kasx3UhJqm3UctG4nzp9tRrekuAVK7DraQHkYn
=============================================================================

8. MINT TOKEN

"spl-token mint kdoVcMtXDdzfDEDSyifG7sLMx6zzpZGD7Hwn5MjoiSs 1000000" 

=============================================================================
output:
-----------------------------------------------------------------------------
Minting 100200300400500 tokens
  Token: kdoVcMtXDdzfDEDSyifG7sLMx6zzpZGD7Hwn5MjoiSs
  Recipient: C1JX4BirMpnzZxKR2VjB4vnTAudqUsJkcnc9aLjpB6Nj

Signature: 3UxP2yn66JX3TEQBqvcSB7HcxKwDPU4AHM7D2WSpnRjVP2WygKRrp89iUjnrWthViqa5MvLN6WoA7bRj5wZUgi5M
=============================================================================

9. REGIST TOKEN 

- Buka file deploy.ts, paste token address di Line 20
=============================================================================
    const mint = new web3.PublicKey("paste token address disini")
=============================================================================

- Ganti Nama Token & Symbol di Line 40
=============================================================================
        name: "MICIN Token",
        symbol: "MICIN",        
=============================================================================

10. SETUP METADATA IMAGE

- Buka "https://token-creator-lac.vercel.app/uploader"
- Konek pake wallet utama (paste privatekey di phantom wallet)
- Bagian Bundler pilih devnet dan konek
- Upload logo token di image URL, signature & ambil linknya 

- Buka metadata.json
- samain data tokennya & paste link logo di "image"

=============================================================================

11. SETUP METADATA.JSON

- Balik lagi ke web tadi, upload file "metadata.json"
- signature & ambil linknya
- paste link metadata tadi ke deploy.ts di line 42 & save (ctrl + s)

=============================================================================
output:
-----------------------------------------------------------------------------
uri: "https://uxm26fljyvkiy7m45ll3iehqk6jzthykw3eiqasnnmpmbhpbli.arweave.net/pdmvFWnFVIx9nOrXtB-DwV5OZnwq2yIgCTWsewJ3hWs",
=============================================================================

12. DEPLOY

"npx ts-node deploy.ts"

=============================================================================
output:
-----------------------------------------------------------------------------
gasskeun
9LSj1J1LCJAuEAALJJiUk24JJZKEakBiwDtMnWnYRHYz
3PnrRwNo6mhzKuWh3he9xbZC9ei6nmHs3T8cS68TF4iJ8koGAxuhLgmafaSgEjtXuNSgHSmwYtqRTw4g6D8nYwDv
=============================================================================


- TAMBAH SUPPLY 

spl-token mint "TOKEN ADDRESS" "JUMLAH YANG MAU DI MINT"
-----------------------------------------------------------------------------
contoh : "spl-token mint 9td35qkU5nPHvcM1siTXtfqXLV5Vo3bve479vBnoZuxa 100000000"
-----------------------------------------------------------------------------



- Fixed Supply 
spl-token authorize "TOKEN ADDRESS" mint --disable
-----------------------------------------------------------------------------
contoh : spl-token authorize 9td35qkU5nPHvcM1siTXtfqXLV5Vo3bve479vBnoZuxa mint --disable
-----------------------------------------------------------------------------

