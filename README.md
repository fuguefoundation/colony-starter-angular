# colony-starter-angular

The goal of this repo is to create a Colony Starter running the Colony Network in Angular. In addition to wanting to understand the power and potential of Decentralized Autonomous Organizations (DAO), and improve my frontend skills, my intent is to give back to these excellent open source projects - and the community at large - that build on top of Ethereum.

![colony-starter-angular](https://github.com/fuguefoundation/colony-starter-angular/blob/master/src/assets/screenshot.png)

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

Incorporate Colony

* These commands are derived from [`initiaze_project.sh`](https://github.com/JoinColony/colonyStarter/blob/master/packages/colony-starter-basic/scripts/initialize_project.sh) script from `colonyStarter`. This part of the setup could be automated, but I doing these commands individually is more useful for understanding the file structure and its submodules.

5. Add colonyNetwork submodule: `git submodule add https://github.com/JoinColony/colonyNetwork src/lib/colonyNetwork`

6. Move to colonyNetwork directory: `cd src/lib/colonyNetwork`

7. Set version of the colonyNework submodule: `git -c advice.detachedHead=false checkout d50abbeb9f119850cb70e9ec854576123a707205`

8. Initialize colonyNetwork submodule: `git submodule update --init --recursive`
* If you get an error here, you might not have [set up your SSH keys](https://help.github.com/articles/connecting-to-github-with-ssh/) for your Github account

9. Install colonyNetwork dependencies: `yarn`

10. Check out this [Issue](https://github.com/fuguefoundation/colony-starter-angular/issues/1) and comment out the three lines of code in the specified .js files in `node_modules`.

## Launch the dApp

Open four terminals. Three should be in the `colonyNetwork` submodule directory (`src/lib/colonyNetwork`), one should be in the project root.

* Colony Network submodule: `ganache-cli -d --gasLimit 7000000 --acctKeys ganache-accounts.json --noVMErrorsOnRPCResponse`
* Colony Network submodule: `./node_modules/.bin/truffle migrate --compile-all --reset` *Make sure Docker is running*
* Colony Network submodule: `trufflepig --ganacheKeyFile ganache-accounts.json`
* Project root: `ng serve`

Navigate to `http://localhost:4200/`. Open the browser console to see the logs. The app will automatically reload if you change any of the source files.

* *To learn more about these steps, refer back to [Colony Starter: Basic](https://github.com/JoinColony/colonyStarter/tree/master/packages/colony-starter-basic)*

## The code

`app.component.ts` is based on some of the examples code from [colony-starter-basic](https://github.com/JoinColony/colonyStarter/tree/master/packages/colony-starter-basic). Colony offers a lot more functionality and capabilities, so start digging into the docs, code, and white paper!

Some key changes made to Angular to get things working:
* `./src/polyfills.js`
    ```
    (window as any).global = window;
    * declare var require: any;
    ```
* `./src/tsconfig.app.json`
    ```
    "compilerOptions": {
        "types": [ "node" ],
        "typeRoots": [ "../node_modules/@types" ]    
    }
    ```
* To get Extended Colony Protocol (ECP), web3, and IPFS to work in Angular, I had to implement the steps [here](https://medium.com/@GrandSchtroumpf/angular-cli-and-web3-e5cb90885741), which involve changes to `angular.json` build and server configuration. More info about Angular and IPFS specifically [here](https://medium.com/@GrandSchtroumpf/ipfs-and-angular-6-6165e6fd6e5d).
    * If you encounter this error: `Cannot read property 'baseHref' of undefined`, see [discussion](https://github.com/angular/angular-cli/issues/10447) here

* Various `colonyJS` packages were added to the `package.json` file generated by Angular-CLI.

## Testing

* Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).
* Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).
* Colony tests: See `package.json` inside `./src/lib/colonyNetork`

## Contributing

See [Issues](https://github.com/fuguefoundation/ng-colony/issues) for bugs. See `CONTRIBUTING.md` for details on pull requests, bug fixes, new features, and such.

## Resources

* [ColonyJS Docs](https://docs.colony.io/colonyjs/docs-overview)
* [Colony Network Docs](https://docs.colony.io/colonynetwork/docs-get-started/)
* [Ganache](https://github.com/trufflesuite/ganache-cli)
* [Truffle Pig](https://github.com/JoinColony/trufflepig)
* [Angular CLI](https://github.com/angular/angular-cli)