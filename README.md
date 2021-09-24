<p align="center"><br><img src="https://avatars3.githubusercontent.com/u/16580653?v=4" width="128" height="128" /></p>

<h3 align="center">Ionic/Vue SQLite Test Issue#172</h3>
<p align="center"><strong><code>vue-test-issue172</code></strong></p>
<p align="center">Ionic/Vue application demonstrating the fix for the</p>
<p align="center"><strong><code>@capacitor-community/sqlite plugin<code></strong></p>
<p align="center" style="font-size:50px;color:red"><strong>CAPACITOR 3 </strong></p><br>
<br>
<p align="center">
  <img src="https://img.shields.io/maintenance/yes/2021?style=flat-square" />
  <a href="https://github.com/jepiqueau/vue-test-issue172"><img src="https://img.shields.io/github/license/jepiqueau/vue-test-issue172?style=flat-square" /></a>
  <a href="https://github.com/jepiqueau/vue-test-issue172"><img src="https://img.shields.io/github/package-json/v/jepiqueau/vue-test-issue172/main?style=flat-square" /></a>
<!-- ALL-CONTRIBUTORS-BADGE:START - Do not remove or modify this section -->
<a href="#contributors-"><img src="https://img.shields.io/badge/all%20contributors-2-orange?style=flat-square" /></a>
<!-- ALL-CONTRIBUTORS-BADGE:END -->
</p>


## Maintainers

| Maintainer        | GitHub                                    | Social |
| ----------------- | ----------------------------------------- | ------ |
| Quéau Jean Pierre | [jepiqueau](https://github.com/jepiqueau) |        |



## Installation 

To start clone the project

```bash
git clone https://github.com/jepiqueau/vue-test-issue172.git
cd ./vue-test-issue172
git remote remove origin
npm install
```


```bash
npm run build 
npx cap sync
```
The `sql-wasm.wasm` file should be copied from `node_modules/sql.js/dist`folder to `public/assets`folder



```bash
npm run build
npx cap copy web
npx run serve
```

## Accessing the tests 
In the browser

```
http://localhost:8080/
```

open the development tool and go into the `console` tab
you should see

```
The testDatabaseNoEncryption was successful
```

## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="https://github.com/jepiqueau"><img src="https://avatars3.githubusercontent.com/u/16580653?v=4" width="100px;" alt=""/><br /><sub><b>Jean Pierre Quéau</b></sub></a><br /><a href="https://github.com/jepiqueau/vue-test-issue172/commits?author=jepiqueau" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/sidquisaad"><img src="https://avatars.githubusercontent.com/u/25284407?v=4" width="100px;" alt=""/><br /><sub><b>Saad Sidqui</b></sub></a><br /><a href="https://github.com/jepiqueau/vue-test-issue172/commits?author=jepiqueau" title="Code">💻</a></td>
    
  </tr>
</table>

<!-- markdownlint-enable -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!

