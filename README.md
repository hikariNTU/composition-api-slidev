[![Build and Deploy](https://github.com/hikariNTU/composition-api-slidev/actions/workflows/main.yml/badge.svg)](https://github.com/hikariNTU/composition-api-slidev/actions/workflows/main.yml)

# Composition API introduction

See the [static deployment](https://hikarintu.github.io/composition-api-slidev).

## What is included?
- [x] p.2) Options API go through 🚗
- [x] p.3) Why Options API is not preferred anymore? 😷
- [x] p.4-5) Composition API rewrite with auto typing! 🎈
- [x] p.6) All-in-one Setup option 🔧
- [x] p.7) Confidence when reusing composable function 🔌
- [x] p.8) Reactive state under the hood ⚙
- [x] p.10) Additional resource from antfu and vue3 community 🎡

## Not going to teach
- [ ] Test composable function (easy-pieces)
- [ ] Best practice of composition api (please look at [Anthony's slide](https://talks.antfu.me/2021/composable-vue/))
- [ ] Go deep into Proxy, Reflect, WeakMap...
- [ ] Using tailwind css atomic
- [ ] How to write React Hook. (Seriously, they are fundamentally different)
- [ ] Making library over 1k stars
- [ ] Making big 💰 with frontend

## Technical Stacks
- Vue3
- Vite(esbuild, rollup)
- Windicss(tailwind)
- Reactive System (with Composition API)
- Slidev
- vue-demi, VueUse

## live mode
To start the slide show:

- `npm install`
- `npm run dev`
- visit http://localhost:3030

This will also enable monaco-editor(vs code) support in browser.

Learn more about Slidev on [documentations](https://sli.dev/).

## PDF?

From slidev documentation:

```
npx slidev export
```
