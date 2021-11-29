# Awesome Internet Computer

This is a directory of all identifiable projects in the Internet Computer ecosystem globally. Its V1.0 was previously hosted on [Github Page](https://zire.github.io/awesome-IC/). Its V2.0 has recently been migrated to Internet Computer - ie. using IC as its backend. 

For Github Page-based V1.0, the deployment workflow goes like:

- Make changes in local machine to `README.md` via `Macdown`, a Markdown editor
- Git all/commit/push
- [Awesome IC](https://zire.github.io/awesome-IC/) will be automatically updated

This workflow ensures version control and what's rendered on Github Page is consistent with the Markdown file.

For IC-based V2.0, the deployment workflow is now:

- Make changes in the local machine via DFN SDK
- Deploy to the canister and the IC website will be updated
- Git all/commit/push to Github repo to back up the code

This workflow loses the link from Github repo to IC site. The consistency between IC site and Github repo is ensured manually, rather by code. It's not perfect, but a small trade-off to bring this useful website to Internet Computer, where it truly belongs.


**How to deploy a static website on Internet Computer**
--

***Step 1: install the dfn SDK***

Go to [dfinity.org](dfinity.org), click on [Developer Center](https://smartcontracts.org/). 

Run this command in the terminal of your local machine to install the sdk. I use `iTerm2` on a Macbook Pro. 

```
sh -ci "$(curl -fsSL https://smartcontracts.org/install.sh)"
```

Here's the screen output:

```
sh -ci "$(curl -fsSL https://smartcontracts.org/install.sh)"
info: Executing dfx install script, commit: 603da2b6c742040cb9d94285dc31813e232804f2
info: Version found: 0.8.4
info: Creating uninstall script in ~/.cache/dfinity
info: uninstall path=/Users/herbert.yang/.cache/dfinity/uninstall.sh
info: Checking for latest release...
Will install in: /usr/local/bin
info: Installed /usr/local/bin/dfx
```

Make sure `brew`, the Mac package manager, and `node` are both installed, by following this [new comer guide](https://smartcontracts.org/docs/quickstart/newcomers.html)

Check `brew` and `node` have been installed properly:

```
brew --version
Homebrew 3.3.4
Homebrew/homebrew-core (git revision 4c66d4547cb; last commit 2021-11-18)
node --version
v16.10.0
```

***Step 2: Create an IC project folder***

On your Github page, create a new repo (can be public or private) `Awesome Internet Computer`

Git clone this repo from Github server to local machine

```
git clone git@github.com:zire/Awesome-Internet-Computer.git
```

Enter into this directory

```
cd Awesome-Internet-Computer
```

Check what are the current directories defined in your environment variable `$PATH`

```
export $PATH
```

Check the location of the `dfx` executable to make sure it's in one of the paths defined in $PATH

```
which dfx
/usr/local/bin/dfx
```

***Step 3: Set up the IC folder***

Follow this guide [hosting a static website on the Internet Computer](https://smartcontracts.org/docs/quickstart/host-a-website.html). 

Right now the folder only has two files, `.git` and `README.md`. Let's create the rest. 

Create `assets` folder, and 4 files inside `assets` folder with `touch` command from `Shell`:

- `index.html`
- `page-2.html`
- `script.js`
- `style.css`

Create some initial contents for this boiler-template, so that the IC site can be launched right away. Once the IC site is live, we can come back and revise all the contents.

I use `Visual Studio Code` for writing HTML files. It's free and easy to use. 

After filling up the above 4 files with initial content, configure DFX to deploy. In the root directory, create a `dfx.jason` and add the following content:

```
{
   "canisters": {
       "website": {
           "type": "assets",
           "source": ["assets"]
       }
   }
}
```

Your directory should look like this now:

```
|---.git
|---README.md
├── assets
│   ├── index.html
│   ├── page-2.html
│   ├── script.js
│   └── style.css
└── dfx.json
```

***Step 4: Set your Cycles wallet address***

You can either use your own Cycles wallet and convert your ICP into Cycles into this wallet, or use 
a wallet with the courtesy of DFINITY and fleek.co that gives you $20.00 Cycles for free.

Follow the guide on [DFINITY Faucet](https://smartcontracts.org/docs/quickstart/cycles-faucet.html), connect your Github account, get your principal ID, and complete the steps until you get to see the "Congrats" screen. You will be given:

- 15 trillion Cycles ("TC") that is worth $20.00
- a Principal ID, `your-principal-id`
- a Wallet ID, `your-wallet-id`

Run the command below in the root directory to set the default wallet for this IC folder

```
dfx identity --network ic set-wallet --force your-wallet-id
Skipping verification of availability of the canister on the network due to --force...
Setting wallet for identity 'default' on network 'ic' to id 'your-wallet-id'
Wallet set successfully.
```
