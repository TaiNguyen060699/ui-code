<script setup>
import { onMounted, ref } from "vue";
const items = ref([
  {
    name: "Vito Corleone",
    popularity: 5,
    biography:
      "Vito Andolini's story starts in Corleone, Sicily. In 1901, the local mafia chieftain, Don Ciccio, murders Vito's father Antonio when he refuses to pay him tribute. Paolo, Vito's older brother, swears revenge, but Ciccio's men kill him too. Ciccio then sends his men to fetch nine-year old Vito. However, Vito's mother insists on going as well and begs Ciccio to spare Vito. Ciccio refuses, reasoning the boy will seek revenge as a grown man. Upon Ciccio's refusal, Vito's mother holds a knife to Ciccio's throat, allowing her son to escape while Ciccio's men kill her. Family friends smuggle Vito out of Sicily, putting him on a ship with immigrants traveling to America. Ellis Island immigration officials rename him Vito Corleone, using his village for his surname. He later uses Andolini as his middle name in acknowledgement of his family heritage.",
    image: "/imgs/vito-corleone.jpg",
    colleagues: ["Carlo Rizzi", "Luci Mancini"],
  },
  {
    name: "Carmelia Corleone",
    popularity: 2,
    biography:
      "Carmela was born in Sicily Italy in 1897, and emigrated to the United States shortly after the turn of the century. She married Vito Corleone in 1914; they were married for just over 40 years until Vito's death in 1955. They had four children – Sonny, Fredo, Michael and Connie. They also took in Sonny's friend Tom Hagen, who later served as the family consigliere. In the novel, Carmela Corleone is portrayed as a traditional Italian immigrant woman who speaks in very broken English. In the movies, however, she speaks fluent English as an adult, with a marked New York accent. In the novel, she develops a close relationship with Michael's girlfriend and future wife, Kay. She is given more expansive dialogue in The Godfather Part II, notably when she confronts her daughter Connie about her behavior early in the film, and when she discusses family life with Michael, who fears that his role as Don of the Corleone criminal empire will cost him his family. Carmela Corleone dies toward the end of the sequel.",
    image: "/imgs/carmelia-corleone.jpg",
    colleagues: [],
  },
  {
    name: "Carlo Rizzi",
    popularity: 5,
    biography:
      "A half northern Italian, half Sicilian native of Nevada and former labourer, Rizzi migrated to New York City following trouble with the law and became a friend of Sonny Corleone, through whom he met Sonny's sister Connie in 1941 at a surprise birthday party for Sonny's father Vito. They were married on the last Saturday of August 1945 in a traditional Italian wedding at the Corleone mall, a compromise made in order to appease Vito, who was disappointed with his daughter's choice in a husband.",
    image: "/imgs/carlo-rizzi.jpg",
    colleagues: ["Vito Corleone", "Carmelia Corleone"],
  },
  {
    name: "Luci Mancini",
    popularity: 5,
    biography:
      "In the novel, Lucy is a fairly important supporting character, with several chapters dedicated to her story. After Sonny's death, Vito's consigliere, Tom Hagen sends Lucy to Las Vegas. She is given a small interest (five and later ten) in one of the family's hotels, primarily so that she can keep an eye on Vito's middle son, Fredo, who is learning the hotel and casino business. She also serves as a shareholder-of-record who has no criminal record: several such owners are necessary for a valid gaming license. On paper she is a millionaire, although she does not vote her shares in the casinos.",
    image: "/imgs/luci-mancini.jpg",
    colleagues: ["Carmelia Corleone"],
  },
]);

const selectedItem = ref(null);

const handleShowContent = (item) => {
  selectedItem.value = item;
};

onMounted(() => {
  selectedItem.value = 0
})
</script>

<template>
  <div class="ui-code">
    <div class="ui-code__wrapper row">
      <div class="ui-code__sidebar col-3">
        <img src="../assets/_logo/the-godfather.svg" alt="" />
        <div v-for="(item, index) in items" :key="index">
          <div class="ui-code__sidebar--title" @click="handleShowContent(index)">
            {{ item.name }}
          </div>
        </div>
      </div>
      <div class="ui-code__content col-9">
        <div class="ui-code__inner">
          <div v-for="(item, index) in items" :key="index" class="ui-code__item">
            <div v-if="selectedItem === index" style="display: flex;">
              <div class="ui-code__image">
                <img :src="item.image" alt="" />
              </div>
              <div v-if="selectedItem === index" class="ui-code__block">
                <div class="ui-code__title">{{ item.name }}</div>
                <div class="ui-code__popularity">
                  <span>Popularity</span>
                  <input type="range" v-model="item.popularity" />
                </div>
                <div class="ui-code__biography">
                  <div>Biography</div>
                  <p>{{ item.biography }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.ui-code {
  width: 100vw;
  height: 100vh;
  background-image: url("../assets/_images/bg-image.jpg");
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  position: relative;

  &__wrapper {
    display: flex;
  }

  &__sidebar {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding: 40px 20px;
    background-color: black;
    height: 100vh;
    opacity: 0.7;

    &--title {
      color: blue;
      font-size: 28px;
      padding: 10px 50px;
      cursor: pointer;

      &:hover {
        font-size: 34px;
        background-color: gray;
      }
    }

    img {
      margin-bottom: 50px;
    }
  }

  &__content {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding: 40px 20px;
  }

  &__title {
    font-size: 28px;
    color: white;
  }

  &__popularity {
    font-size: 16px;
    color: white;
    display: flex;
    align-items: center;

    span {
      padding-right: 20px;
    }

    input[type="range"] {
      /* removing default appearance */
      -webkit-appearance: none;
      appearance: none;
      /* creating a custom design */
      width: 50%;
      cursor: pointer;
      outline: none;
      border-radius: 15px;
      /*  overflow: hidden;  remove this line*/

      /* New additions */
      height: 2px;
      background: black;
    }

    /* Thumb: webkit */
    input[type="range"]::-webkit-slider-thumb {
      /* removing default appearance */
      -webkit-appearance: none;
      appearance: none;
      /* creating a custom design */
      height: 15px;
      width: 15px;
      background-color: black;
      border-radius: 50%;
      border: none;

      /* box-shadow: -407px 0 0 400px #f50; emove this line */
      transition: .2s ease-in-out;
    }

    /* Thumb: Firefox */
    input[type="range"]::-moz-range-thumb {
      height: 15px;
      width: 15px;
      background-color: black;
      border-radius: 50%;
      border: none;

      /* box-shadow: -407px 0 0 400px #f50; emove this line */
      transition: .2s ease-in-out;
    }

    /* Hover, active & focus Thumb: Webkit */

    input[type="range"]::-webkit-slider-thumb:hover {
      box-shadow: 0 0 0 10px rgba(255, 85, 0, .1)
    }

    input[type="range"]:active::-webkit-slider-thumb {
      box-shadow: 0 0 0 13px rgba(255, 85, 0, .2)
    }

    input[type="range"]:focus::-webkit-slider-thumb {
      box-shadow: 0 0 0 13px rgba(255, 85, 0, .2)
    }

    /* Hover, active & focus Thumb: Firfox */

    input[type="range"]::-moz-range-thumb:hover {
      box-shadow: 0 0 0 10px rgba(255, 85, 0, .1)
    }

    input[type="range"]:active::-moz-range-thumb {
      box-shadow: 0 0 0 13px rgba(255, 85, 0, .2)
    }

    input[type="range"]:focus::-moz-range-thumb {
      box-shadow: 0 0 0 13px rgba(255, 85, 0, .2)
    }
  }

  &__inner {
    padding: 200px;
  }

  &__item {
    display: flex;
  }

  &__image {
    margin-right: 40px;

    img {
      width: 150px;
      height: 150px;
    }
  }

  &__popularity {
    margin: 20px 0;
  }

  &__biography {
    padding: 20px;
    background-color: black;
    color: white;

    div {
      font-weight: 700;
      margin-bottom: 10px;
    }
  }
}
</style>
