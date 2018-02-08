# Ethereum Mining on Amazon AWS

In short, ethereum mining on Amazon AWS is not profitable. However, if you are interested in ethereum mining, the following content would be a good tutorial.

## 1 Setup your ETH wallet

There are plenty of choices for ETH wallet, take a look at this review and setup your own wallet address.

<a href="https://coinsutra.com/best-etherum-wallets/" target="_blank">The Top 10 Best Ethereum Wallets (2018 Edition)</a>

## 2 Request spot instance

The instances with high-performance GPU are in type `p2, p3, g2, g3`.

In `Security Groups` settings, open port 22 for SSH connection, and open both  UDP and TCP connection on port 30303 for mining.

For `AMI`, choose `Canonical, Ubuntu, 16.04 LTS`.

## 3 Install software

Update available package list:

`$ sudo apt-get update`

Upgrade installed packages:

`$ sudo apt-get upgrade` 

Install the required drivers for your video card:

`$ sudo apt-get install nvidia-cuda-toolkit`

Install tmux, your miner will continue working after you logout SSH:

`$ sudo apt-get install tmux`

Download the latest version of ethminer:

`$ wget https://github.com/ethereum-mining/ethminer/releases/download/v0.14.0.dev1/ethminer-0.14.0.dev1-Linux.tar.gz`

Extract file:

`$ tar zxvf ethminer-0.14.0.dev1-Linux.tar.gz`

Change to the directory with executable miner file, and start mining.

Here, I choose <a href="https://ethermine.org/" target="_blank"> ethermine.org</a> pool, which is the largest ETH mining pool at this time.

```
$ cd bin/
$ ./ethminer --farm-recheck 200 -U -S us1.ethermine.org:4444 -FS us1.ethermine.org:14444 -O 7B1a81A6E4F62055f9c1b7d6CA15e41caa6e0663
```

Notice `7B1a81A6E4F62055f9c1b7d6CA15e41caa6e0663` should be replaced by your ethereum address.

- `--farm-recheck` determines how often to check for work
- `-U` says to use CUDA, if you want to use OpenCL, replace it with `-G`
- `-S/--stratum` and `-FS/--failover-stratum` are the remote nodes I connect to
- replace `7B1a81A6E4F62055f9c1b7d6CA15e41caa6e0663` with your own ethereum address after `-O`

After a moment, you can monior your mining status here:

<a href="https://ethermine.org/miners/7B1a81A6E4F62055f9c1b7d6CA15e41caa6e0663" target="_blank">https://ethermine.org/miners/7B1a81A6E4F62055f9c1b7d6CA15e41caa6e0663</a>

## 4 Comparison

| Instance type | GPU type | # of GPUs | Hash rate | Spot price (USD) | Annual price (USD) |
| :--: | :--: | :--: | :--: | :--: | :--: |
| g2.2xlarge | NVIDIA GRID K520 | 1 | 4.8 Mh/s/GPU | 0.204 /h | 372.30 /Mh/s |
| g3.4xlarge | NVIDIA Tesla M60 | 1 | 8.1 Mh/s/GPU | 0.4302 /h | 465.25 /Mh/s |
| p2.8xlarge | NVIDIA Tesla K80 | 8 | 7 Mh/s/GPU | 2.16 /h | 337.89 /Mh/s |
| p3.2xlarge | NVIDIA Tesla V100 | 1 | 94.8 Mh/s/GPU | 1.2733 /h | 117.66 /Mh/s |
