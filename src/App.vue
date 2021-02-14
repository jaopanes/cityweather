<template>
    <div id="app">
        <h1>City<span>Weather</span></h1>

        <div class="input-group">
            <label for="search">Pesquise sua cidade</label>
            <input
                type="text"
                id="search"
                v-model="inputSearch"
                @change="search"
            />
        </div>

        <City v-show="showCity" :data="city" />
    </div>
</template>

<script>
import axios from "axios";
import City from "./components/City";

export default {
    name: "App",

    data() {
        return {
            city: {
                name: "",
                temp: "",
                icon: "",
                cond: "",
            },
            inputSearch: "",
            showCity: false,
        };
    },

    components: {
        City,
    },

    methods: {
        search: async function () {
            if (this.inputSearch.lenght != "") {
                axios
                    .get(
                        `https://api.openweathermap.org/data/2.5/weather?q=${this.inputSearch}&lang=pt_br&units=metric&appid=${process.env.VUE_APP_OPENWEATHER_APPID}`
                    )
                    .then((response) => {
                        this.city.name = response.data.name;
                        this.city.temp = response.data.main.temp;
                        this.city.icon =
                            "http://openweathermap.org/img/wn/" +
                            response.data.weather[0].icon +
                            "@2x.png";
                        this.city.cond = response.data.weather[0].main;

                        this.showCity = true;
                    });
            }
        },
    },
};
</script>

<style>
h1 {
    font-weight: bold;
    font-size: 48px;
    color: #1d365a;
    text-transform: uppercase;
}
h1 span {
    color: #1b76ff;
}
.input-group {
    width: 345px;
    position: relative;
    margin-top: 25px;
    margin-bottom: 70px;
}
input {
    width: 100%;
    height: 60px;
    background: #ffffff;
    box-shadow: 0px 4px 10px rgba(29, 54, 90, 0.08);
    border-radius: 10px;
}
label {
    font-weight: 300;
    font-size: 16px;
    color: rgba(29, 54, 90, 0.61);
    margin-bottom: 10px;
    display: block;
}
</style>
