# SpeedSouls

![deploy_prod](https://github.com/CapitaineToinon/SpeedSouls/workflows/deploy_prod/badge.svg)
![deploy_dev](https://github.com/CapitaineToinon/SpeedSouls/workflows/deploy_dev/badge.svg)

## Project setup
Install dependencies
```
yarn install
```
Download games' backgrounds (only need to do it once). We don't use this for DrakeNieR's site.
```
node ./scripts/downloadBackgrounds.js
```
Then start the development server
```
yarn serve
```
## Compiles and minifies for production
```
yarn build
```

## Lints and fixes files
```
yarn lint
```
