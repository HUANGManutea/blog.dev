---
title: "Payzen e-shopping formulaire - Inventaire"
date: 2022-05-16T21:49:19-10:00
draft: false
tags: [Payzen, Web, Node.js, Next.js]
categories: [Tutoriel]
---
Cet article fait partie d'une suite de tutoriels d'intégration Payzen dans une application web d'e-shopping. Vous trouverez le précédent article [ici](https://huangmanutea.github.io/blog.dev/posts/payzen_e-shopping_formulaire/introduction/).

# Introduction

L'une des composantes principales d'une application de e-shopping est d'avoir une base de données de produits.

Chaque produit possède différentes propriétés, comme le prix à l'unité et le nom du produit.

Afin de nous focaliser sur le paiement, nous n'allons pas créer de base de données, nous n'allons pas implémenter une API, ni faire d'appel d'API.

Nous allons uniquement instancier une liste d'objets *produits* en guise d'inventaire.


# User Story

1. En tant qu'**utilisateur**
2. Je veux **voir tous les produits que je peux acheter**
3. Afin de **choisir le produit que je veux acheter**

# Création de l'inventaire

Dans pages/index.js, créer l'inventaire dans la fonction **getServerSideProps** comme suit:

```react
// pages/index.js
export async function getServerSideProps() {
  // for tutorial purposes, easier to understand than a loop
  const data = {
    inventory: [
      {
        id: 1,
        name: "article 1",
        price: 1000
      },
      {
        id: 2,
        name: "article 2",
        price: 2000
      },
      {
        id: 3,
        name: "article 3",
        price: 3000
      },
      {
        id: 4,
        name: "article 4",
        price: 4000
      },
      {
        id: 5,
        name: "article 5",
        price: 5000
      },
      {
        id: 6,
        name: "article 6",
        price: 6000
      }
    ]
  }

  // Pass data to the page via props
  return { props: { data } }
}
...
```
Ce qui nous permettra ensuite de récupérer l'inventaire dans la page de cette façon

```react
// pages/index.js
...
export default function Home({ data }) {
  console.log(data.inventory)
  return (
    <div className="container">
      <Head>
        <title>Tutoriel Payzen e-shopping</title>
        <link rel="icon" href="/favicon.ico" />
      </Head>

      <main>
        <h1 className="title">
          Welcome to <a href="https://nextjs.org">Next.js!</a>
        </h1>
      </main>

      <style jsx global>{`
      `}</style>
    </div>
  )
}
```

Sur le site (dans votre navigateur), si vous ouvrez les DevTools (F12 pour Windows), vous verez l'inventaire.

![Inventaire](inventory.png#center "Inventaire")

# Affichage

Nous allons maintenant afficher l'inventaire sur la page.

Tout d'abord nous devons créer un composant **Item**

```bash
mkdir components
touch components/item.js
```

```react
// components/item.js
export default function Item({item}) {

  const buy = () => {
    console.log(item)
  }

  return (
    <div className="bg-white shadow overflow-hidden sm:rounded-lg hover:opacity-75 cursor-pointer" onClick={buy}>
      <div className="flex flex-col px-4 py-5 sm:px-6">
        <div className="flex flex-row gap-1">
          <h2>Name:</h2>
          <p>{item.name}</p>
        </div>
        <div className="flex flex-row gap-1">
          <h2>Price:</h2>
          <p>{item.price} <span>XPF</span></p>
        </div>
      </div>
    </div>
  )
}
```

Il devrait ressembler à ça:

![Item](item.png#center "Item")

Nous implémenterons la fonction **buy** dans un autre article.

Nous devons ensuite transformer l'inventaire en composants **Item**, pour pouvoir l'afficher dans la page **index.js**.

```react
// pages/index.js
import Head from 'next/head'
import Item from '../components/item'

export async function getServerSideProps() {
  // for tutorial purposes, easier to understand than a loop
  const data = {
    inventory: [
      {
        id: 1,
        name: "article 1",
        price: 1000
      },
      {
        id: 2,
        name: "article 2",
        price: 2000
      },
      {
        id: 3,
        name: "article 3",
        price: 3000
      },
      {
        id: 4,
        name: "article 4",
        price: 4000
      },
      {
        id: 5,
        name: "article 5",
        price: 5000
      },
      {
        id: 6,
        name: "article 6",
        price: 6000
      }
    ]
  }

  // Pass data to the page via props
  return { props: { data } }
}

export default function Home({ data }) {
  return (
    <div className="flex flex-col p-2">
      <Head>
        <title>Tutoriel Payzen e-shopping</title>
        <link rel="icon" href="/favicon.ico" />
      </Head>

      <main>
        <div className='flex flex-row content-center justify-center'>
          <div className='flex flex-col content-center justify-center gap-2'>
            <h1 className="font-bold text-lg text-gray-600 text-center">Boutique</h1>
            <div className='grid grid-cols-4 grid-flow-row gap-2'>
              {data.inventory.map((item, i) => <Item key={i} item={item}/>)}
            </div>
          </div>
        </div>
      </main>
    </div>
  )
}
```

Vous devriez maintenant avoir cet affichage

![Boutique](boutique.png#center "Boutique")

En cliquant sur l'un des **Item**, vous verrez apparaître dans la console, l'objet item associé.

# Conclusion

Nous venons d'implémenter une liste de produits et de l'afficher. Nous venons également de préparer la sélection de l'article à acheter.

Dans le prochain article, nous verrons comment transformer cette sélection d'article en paiement.