---
sidebar_position: 2
---

# Installation

:::warning READ BEFORE PROCEEDING!
We've spent hours making this documentation. You're supposed to at least have basic linux knowledge, and you're also supposed to understand what commands you're running.
:::

## Supported Operating Systems
|    Name     |   Versions    |
|-------------|---------------|
|   [Ubuntu](#ubuntu-and-debian)    |    >=20.04    |
|   [Debian](#ubuntu-and-debian)    |    >=10       |
|   [Windows](#windows)   |    >=10.x     |
|   CentOS    |  Coming Soon  |


Before you begin installation, make sure you have NodeJS v14 or above, git CLI, and Node Package Manager (NPM) v7.x or above installed.

## Ubuntu and Debian
Firstly, make sure that you have all the prerequisites above installed (if you do you can skip this part).

```bash
sudo apt update && sudo apt upgrade

# installing git CLI
sudo apt install git

# installing MySql
sudo apt install mariadb-server

# installing NPM
sudo apt install npm

# installing NodeJS
curl -fsSL https://deb.nodesource.com/setup_14.x | sudo bash -
sudo apt install nodejs
```

You can check the versions with the following commands:
```bash
git --version
npm -v
node -v
```

Now to install Faliactyl and its dependencies:
```bash
git clone https://github.com/Hyricon-Development/Faliactyl.git
cd Faliactyl && npm install
```

After installing Faliactyl, Go to `settings.json`

## Windows
First, make sure you have all the prerequisites listed at the top of the page (if you do you can skip this part).

- Git CLI: https://git-scm.com/download/win
- NPM and NodeJS: https://nodejs.org/en/

You can check the versions with the following commands:
```bat
git --version
npm -v
node -v
```

Now to install Faliactyl and its dependencies:
```bat
git clone https://github.com/Hyricon-Development/Faliactyl.git
cd Faliactyl && npm install
```

After installing Faliactyl, Go to `settings.json`

---

Once you have configured your `settings.json` file you can run Faliactyl with `node .` or an external module such as PM2.
