<template>
  <div class="grid mt-1 xl:mt-7">
  <div class="col-12">
    <h1 class="text-center text-white text-2xl" id="header-text">Escoge una tarjeta</h1>
  </div>
    <div class="col-6 xl:col-3 flip-card" id="card">
      <div class="flip-card-inner">
        <div class="flip-card-front">
          <img src="../assets/img/question-mark.png" class="question-mark" alt="question-mark" />
        </div>
        <div class="flip-card-back belgica">
          <div class="blur">
            <h1>Bruselas</h1>
            <figure>
              <div>
                <img src="../assets/img/belgium.svg" class="flag">
              </div>
            </figure>
          </div>
        </div>
      </div>
    </div>
    <div class="col-6 xl:col-3 flip-card" id="card">
      <div class="flip-card-inner">
        <div class="flip-card-front">
          <img src="../assets/img/question-mark.png" class="question-mark" alt="question-mark" />
        </div>
        <div class="flip-card-back alemania">
          <div class="blur">
            <h1>Berlin</h1>
            <figure>
              <div>
                <img src="../assets/img/germany.svg" class="flag">
              </div>
            </figure>
          </div>
        </div>
      </div>
    </div>
    <div class="col-6 xl:col-3 flip-card" id="card">
      <div class="flip-card-inner">
        <div class="flip-card-front">
          <img src="../assets/img/question-mark.png" class="question-mark" alt="question-mark" />
        </div>
        <div class="flip-card-back irlanda">
          <div class="blur">
            <h1>Dublin</h1>
            <figure>
              <div>
                <img src="../assets/img/ireland.svg" class="flag">
              </div>
            </figure>
         </div>
        </div>
      </div>
    </div>
    <div class="col-6 xl:col-3 flip-card" id="card">
      <div class="flip-card-inner">
        <div class="flip-card-front">
          <img src="../assets/img/question-mark.png" class="question-mark" alt="question-mark" />
        </div>
        <div class="flip-card-back escocia">
          <div class="text-xs blur">
            <h1>Edimburgo</h1>
            <figure>
              <div>
                <img src="../assets/img/scotland.svg" class="flag">
              </div>
            </figure>
          </div>
        </div>
      </div>
    </div>

    <div v-if="clicked && selectedCountry == 'belgica'" class="col-8">
      <img src="../assets/img/mapa_espana_belgica.png" class="map">
      <img src="../assets/img/plane.png" class="plane-belgium">
    </div>
    <div v-if="clicked && selectedCountry == 'alemania'" class="col-8">
      <img src="../assets/img/mapa_espana_alemania.png" class="map">
      <img src="../assets/img/plane.png" class="plane-germany">
    </div>
    <div v-if="clicked && selectedCountry == 'irlanda'" class="col-8">
      <img src="../assets/img/mapa_espana_irlanda.png" class="map">
      <img src="../assets/img/plane.png" class="plane-ireland">
    </div>
    <div v-if="clicked && selectedCountry == 'escocia'" class="col-8">
      <img src="../assets/img/mapa_espana_escocia.png" class="map-scotland">
      <img src="../assets/img/plane.png" class="plane-scotland">
    </div>
  </div>
</template>

<script setup>

import { ref, onMounted } from 'vue';

const clicked = ref(false);

const selectedCountry = ref(null);

onMounted(() => {
  const cards = document.querySelectorAll("#card");

  cards.forEach((card) => {
    card.addEventListener('click', () => {
      card.classList.toggle('clicked');
      selectedCountry.value = selectedCountry.value == null ? (card.childNodes[0].childNodes[1]).classList[1] : null;
      clicked.value = !clicked.value;
      document.getElementById('header-text').innerHTML = clicked.value ? `¡Nos vamos a ${(selectedCountry.value).charAt(0).toUpperCase() + (selectedCountry.value).slice(1)}! 🛩️` : 'Escoge una tarjeta';
      document.getElementById('header-text').classList.toggle('text-left');
      document.getElementById('header-text').classList.toggle('ml-5');
      cards.forEach((c) => {
        if (c !== card) {
          c.classList.toggle('unclicked');
        }
      })
    });
  })
})
</script>

<style lang="scss" scoped>
.belgica, .alemania, .irlanda, .escocia {
  height: 100%;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  z-index: -100;
}

.flag {
  width:280px;
  height: 150px;  
}

.map {
  position: absolute;
  top: 50%;
  left: 60%;
  transform: translate(-50%, -50%);
  width: 40%;
}

.map-scotland {
  position: absolute;
  top: 50%;
  left: 60%;
  transform: translate(-50%, -50%);
  width: 30%;
}

.plane-belgium {
  position: absolute;
  top: 45%;
  left: 64%;
  transform: translate(-50%, -50%) rotate(-15deg);
  width: 8%;
}
.plane-germany {
  position: absolute;
  top: 68%;
  left: 54%;
  transform: translate(-50%, -50%) rotate(-15deg);
  width: 5.5%;
}
.plane-ireland {
  position: absolute;
  top: 48%;
  left: 64%;
  transform: translate(-50%, -50%) rotate(-55deg);
  width: 10%;
}

.plane-scotland {
  position: absolute;
  top: 68%;
  left: 54%;
  transform: translate(-50%, -50%) rotate(-35deg);
  width: 10%;
}

.belgica {
  background-image: url("../assets/img/bruselas.jpg");
}

.alemania {
  background-image: url("../assets/img/berlin.jpg");
}
.irlanda {
  background-image: url("../assets/img/dublin.jpg");
}
.escocia {
  background-image: url("../assets/img/edimbourg.jpg");
}

.unclicked {
  /* visibility: hidden; */
  display: none;
}



@media screen and (max-width: 768px) {
  .belgica, .alemania, .irlanda, .escocia {
    height: 100%;
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
    z-index: -100;
  }

  .flag {
    width:7rem;
    height: 4rem;
    padding: 0;
    margin-left: -1.3rem;
  }

  .map {
    position: absolute;
    top: 80%;
    left: 60%;
    transform: translate(-50%, -50%);
    width: 80%;
  }

  .map-scotland {
    position: absolute;
    top: 75%;
    left: 60%;
    transform: translate(-50%, -50%);
    width: 80%;
  }

  .plane-belgium {
    position: absolute;
    top: 80%;
    left: 64%;
    transform: translate(-50%, -50%) rotate(-15deg);
    width: 18%;
  }
  .plane-germany {
    position: absolute;
    top: 89%;
    left: 44%;
    transform: translate(-50%, -50%) rotate(-9deg);
    width: 12%;
  }
  .plane-ireland {
    position: absolute;
    top: 81%;
    left: 65%;
    transform: translate(-50%, -50%) rotate(-55deg);
    width: 10%;
  }

  .plane-scotland {
    position: absolute;
    top: 84%;
    left: 45%;
    transform: translate(-50%, -50%) rotate(-35deg);
    width: 20%;
  }
  .belgica {
    background-image: url("../assets/img/bruselas.jpg");
  }

  .alemania {
    background-image: url("../assets/img/berlin.jpg");
  }
  .irlanda {
    background-image: url("../assets/img/dublin.jpg");
  }
  .escocia {
    background-image: url("../assets/img/edimbourg.jpg");
  }
}
</style>
