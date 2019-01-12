# colony-starter-angular

The goal of this repo is to create a Colony Starter running the Colony Network in Angular. In addition to wanting to understand the power and potential of Decentralized Autonomous Organizations (DAO), and improve my frontend skills, my intent is to give back to these excellent open source projects - and the community at large - that build on top of Ethereum.

## Prerequisites
* Yarn 1.12.3
* Docker
* Node 10.12.0
* Angular CLI

## Setup

1. Clone repo: `git clone https://github.com/fuguefoundation/colony-starter-angular.git`
2. `cd colony-starter-angular`
3. `npm install`

Incorporate Docker

4. `docker pull ethereum/solc:0.4.23`
* Be sure Docker is running

Incorporate Colony

* Commands pulled from `initiaze_project.sh` script in XXX. This may be automated in a future update, but I personally believe doing these commands individually is more educational.

// Add colonyNetwork submodule
5. `git submodule add https://github.com/JoinColony/colonyNetwork src/lib/colonyNetwork`

// Move to colonyNetwork directory
6. `cd src/lib/colonyNetwork`

// Set colonyNework version
7. `git -c advice.detachedHead=false checkout d50abbeb9f119850cb70e9ec854576123a707205`

// Initialize colonyNetwork submodule
8. git submodule update --init --recursive
* If you get an error here, you might not have [set up your SSH keys](https://help.github.com/articles/connecting-to-github-with-ssh/) for your Github account

// Install colonyNetwork dependencies
9. `yarn`

## Launch the dApp

Open four terminals. Three should be in the `colonyNetwork` submodle (`src/lib/colonyNetwork`), one should be in the project root.

* Colony Network submodule: `ganache-cli -d --gasLimit 7000000 --acctKeys ganache-accounts.json --noVMErrorsOnRPCResponse`
* Colony Network submodule: `./node_modules/.bin/truffle migrate --compile-all --reset` *Make sure Docker is installed and running*
* Colony Network submodule: `trufflepig --ganacheKeyFile ganache-accounts.json`
* Project root: `ng serve`

Navigate to `http://localhost:4200/`. Open the browser console to see the logs. The app will automatically reload if you change any of the source files.

* *To learn more about these steps, study [Colony Starter: Basic](https://github.com/JoinColony/colonyStarter/tree/master/packages/colony-starter-basic)*

## The code

`app.component.ts` is based on some of the sample code from [colonyjs get started docs](https://docs.colony.io/colonyjs/docs-get-started/). Colony offers a lot more functionality and capabilities, so start digging into the docs and white paper!

Some key changes made to Angular to get things working:
* `.src/polyfills.js`
    ```
    (window as any).global = window;
    * declare var require: any;
    ```
* `.src/tsconfig.app.json`
    ```
    "compilerOptions": {
        "types": [ "node" ],
        "typeRoots": [ "../node_modules/@types" ]    
    }
    ```
* To get Extended Colony Protocol (ECP), web3, and IPFS to work in Angular, I had to implement the steps [here](https://medium.com/@GrandSchtroumpf/angular-cli-and-web3-e5cb90885741), which involve changes to `angular.json` build and server configuration. More info about Angular and IPFS specifically [here](https://medium.com/@GrandSchtroumpf/ipfs-and-angular-6-6165e6fd6e5d).
    * [Discussion](https://github.com/angular/angular-cli/issues/10447), if you encounter this error: `Cannot read property 'baseHref' of undefined`

* Various `colonyJS` packages were added to `package.json`


## Testing

* Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).
* Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/). Make sure you are serving the app via `ng serve`.
* Colony tests using Jest - `npm run colony-test`

## TODO

## Contributing

See [Issues](https://github.com/fuguefoundation/ng-colony/issues) for bugs. See `CONTRIBUTING.md` for details on pull requests, bug fixes, new features, and such.

## Resources

* [ColonyJS Docs](https://docs.colony.io/colonyjs/docs-overview)
* [Colony Network Docs](https://docs.colony.io/colonynetwork/docs-get-started/)
* [Ganache](https://github.com/trufflesuite/ganache-cli)
* [Truffle Pig](https://github.com/JoinColony/trufflepig)
* [Angular CLI](https://github.com/angular/angular-cli)

## Notes

1. To get Extended Colony Protocol (ECP) to work in Angular, I had to implement the steps [here](https://medium.com/@GrandSchtroumpf/angular-cli-and-web3-e5cb90885741)