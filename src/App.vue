<script>
import axios from "axios";
export default {
    data() {
        return {
            city: "",
            error: "",
            info: null
        }
    },
    computed: {
        cityName() {
            return "«" + this.city + "»"
        },
        showTemp() {
            return "Температура: " + this.info.main.temp
        },
        showFeelsLike() {
            return "Температура: " + this.info.main.feels_like
        },
        showMinTemp() {
            return "Температура: " + this.info.main.temp_min
        },
        showMaxTemp() {
            return "Температура: " + this.info.main.temp_max
        },
    },
    methods: {
        getWeather() {
            if (this.city.trim().length < 3) {
                this.error = "Нужно название больше 2 симолов"
                return false
            }
            this.error = ""
            this.info = null
            axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=3d9de74844d28377e81415151cbe6a66`)
                .then(res => (this.info = res.data))
                .catch(error => (this.error = error.message))
        }
    }
}
</script>`
<template>
    <div className="wrapper">
        <h1>Погодное приложение</h1>
        <p>Узнать погоду в <br> {{ city === "" ? "вашем городе" : cityName }}</p>
        <div className="form-wrap">
            <div class="input-wrap">
                <input v-model="city" type="text" placeholder="Введите город" name="city">
            </div>
            <button v-if="city !==''" type="button" @click="getWeather()">Получить погоду</button>
            <button disabled style="pointer-events: none" v-else type="button">Введите название города</button>
        </div>
        <p className="error">{{ error }}</p>
        <div v-if="info !== null" className="info">
            <p>Температура: {{ showTemp }}</p>
            <p>Ощущается как: {{ showFeelsLike }}</p>
            <p>Минимальная температура: {{ showMinTemp }}</p>
            <p>Максимальная температура: {{ showMaxTemp }}</p>
        </div>
    </div>

</template>

<style scoped>
p {
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
    text-overflow: ellipsis;
    word-break: break-word;
}
.wrapper {
    background-color: #333;
    padding: 20px;
    border-radius: 20px;
    text-align: center;
    height: 500px;
}

.wrapper h1 {
    margin-top: 50px;
}

.form-wrap {
    position: relative;
    display: flex;
    justify-content: center;
    gap: 20px;
    margin-top: 30px;
}

.form-wrap button {
    padding: 14px 16px;
    background-color: var(--second-color);
    border: none;
    outline: none;
    border-radius: 20px;
    cursor: pointer;
    transition: padding 0.3s ease-in-out, background-color 0.5s ease-in-out, transform 0.3s ease-in-out;
    border-bottom: 1px solid transparent;

}

.form-wrap button:hover {
    transform: scale(1.05);
    background-color: var(--first-color);
    border-bottom: 1px solid var(--second-color);
}

.form-wrap input {
    position: relative;
    padding: 14px 22px;
    background-color: #222222;
    border-radius: 20px;
    outline: none;
    border: none;
    transition: background-color .2s ease-in-out;
    border-bottom: 1px solid transparent;

}

.form-wrap input:focus {
    border-bottom: 1px solid darkmagenta;
    background-color: #111;
}
.error {
    margin-top: 16px;
    color: #dd3333;
}
.info {
    display: flex;
    flex-direction: column;
    gap: 30px;
}


</style>

