<template>
  <header>
    <div class="logo">
      <div class="circle">
        <a href="#main">
          <img src="/static/svg/logo-busnack-header.svg" alt="Logo Busnack" />
        </a>
      </div>
    </div>

    <ul class="navbar">
      <li v-for="(section, i) of sections" :key="i">
        <a class="bus-link" :href="`#${section.href}`">
          <h3 v-text="section.name"></h3>
        </a>
      </li>
    </ul>
  </header>

  <main id="main">
    <div class="content">
      <h1>
        Tu viaje puede ser<br />
        aún más <span class="unset">Refrescante.</span>
      </h1>
      <p class="unset">
        Prueba Busnack y convierte tus viajes en una<br />
        experiencia más deliciosa
      </p>
    </div>
  </main>

  <section id="product">
    <div class="bus-content">
      <h3>El Producto</h3>
      <h2>Te presentamos Busnack</h2>
      <p>
        Con nuestra aplicación web, ahora tus pasajeros podrán una experiencia a bordo más
        variada y con una rica amplia selección de sabores. Busnack permite digitalizar,
        agilizar y automatizar la venta de alimentos y bebidas dentro de los buses, a
        través de la implementación de una carta digital y auxiliar en el bus.
      </p>

      <div class="images">
        <img src="/static/img/features-row1.png" alt="Caracteristicas fila 1" />
        <img src="/static/img/features-row2.png" alt="Caracteristicas fila 2" />
      </div>
    </div>

    <img src="/static/img/menu-busnack.png" alt="Bus de Pullman Bus" />
  </section>

  <section id="menu">
    <img src="/static/img/menu-phone.png" alt="Smartphone mostrando el menu de Busnack" />

    <div class="bus-content">
      <h3>El Menú</h3>
      <h2>Una rica variedad digital</h2>
      <p>
        Los viajes ahora serán una experiencia llena de sabores: chocolates, papas fritas,
        galletas, frutos secos y por supuesto, bebidas refrescantes para acompañar todo lo
        que desees probar. Escoge el sabor con el que deseas acompañar tu viaje y olvídate
        de hacer largas filas en las tiendas de la estación.
      </p>

      <carousel :settings="settings">
        <slide v-for="(menu, i) of [...menuList, '']" :key="i" class="card">
          <div class="content">
            <div
              class="card-image"
              :style="{ backgroundImage: `url('/static/img/menu/menu-${i + 1}.png')` }"
            ></div>
            <p v-html="menu"></p>
          </div>
        </slide>
        <slide class="card"></slide>

        <template #addons>
          <navigation />
        </template>
      </carousel>

      <div class="container-btn">
        <button class="bus-btn" @click="goTo('https://pullman.busnack.cl/')">
          <span>Conoce nuestro menú</span>
        </button>
      </div>
    </div>
  </section>

  <section id="about">
    <div class="bus-content">
      <h3>Nosotros</h3>
      <h2>Más de 1.000 personas han disfrutado de Busnack</h2>
      <p>
        Del Norte al Sur, hemos elevado la experiencia de viajes a lo largo de todo Chile
        con un rica selección de sabores dulces y salados para complacer el paladar del
        viajero. Para disfrutar de Busnack solo deberás: Visualizar el menú, escoger los
        productos, llamar al auxiliar (Haz tu pedido) y reciber el pedido en tu asiento,
        sin contacto, arriba del bus y completamente digital ¡Así de sencillo!
      </p>
    </div>

    <img src="/static/img/pullman-bus.png" alt="Bus de Pullman Bus" />
  </section>

  <div id="banner-end">
    <div class="container-banner">
      <div class="bus-content">
        <h2>¿Ya usaste Busnack? ¡Déjanos saber tu opinión!</h2>
        <p>Llenar nuestra encuesta tan solo te tomará 3 minutos</p>

        <button class="bus-btn" @click="goTo('https://forms.gle/DpQQGrnfN9fioYTN6')">
          <span>Ir a la encuesta</span>
        </button>
      </div>
    </div>
  </div>

  <footer>
    <div class="data">
      <p>Ubicación:</p>
      <p>Los Conquistadores 2440, Providencia,<br />Región Metropolitana.</p>
    </div>

    <img src="/static/svg/logo-busnack-footer.svg" alt="Logo Busnack" />

    <div class="data">
      <p>Un Producto desarrollado por</p>
      <img src="/static/svg/logo-wit.svg" alt="Logo WIT" />
    </div>
  </footer>
</template>

<script>
import { onMounted } from 'vue'
import { Carousel, Slide, Navigation } from 'vue3-carousel'
import 'vue3-carousel/dist/carousel.css'

const sections = [
  {
    name: 'El producto',
    href: 'product'
  },
  {
    name: 'El menú',
    href: 'menu'
  },
  {
    name: 'Nosotros',
    href: 'about'
  },
  {
    name: '¿Ya lo probaste?',
    href: 'banner-end'
  }
]
const menuList = [
  'Papas fritas<br />Lays',
  'Barra de cereal<br />Fruta Yoghurt',
  'Brownie<br />Nutra bien',
  'Alfajor<br />Nutra Bien',
  'Coca-Cola',
  'Jugo Andina'
]
const settings = {
  itemsToShow: 4.5,
  itemsToScroll: 4,
  // wrapAround: true,
  snapAlign: 'end'
}

export default {
  name: 'App',

  components: {
    Carousel,
    Slide,
    Navigation
  },
  methods: {
    goTo(link) {
      window.open(link)
    }
  },
  setup() {
    onMounted(() => {
      const navbar = document.querySelectorAll('a[href^="#"]')

      navbar.forEach(link => {
        link.addEventListener('click', e => {
          e.preventDefault()

          const hrefID = link.getAttribute('href').replace('#', '')
          const section = document.getElementById(hrefID)

          scrollTo({
            top: section.offsetTop - 30,
            behavior: 'smooth'
          })
        })
      })
    })

    return {
      sections,
      menuList,
      settings
    }
  }
}
</script>

<style lang="scss" src="./scss/main.scss" />
