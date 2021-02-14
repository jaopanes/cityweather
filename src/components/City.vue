<template>
    <article :class="data.cond | lower">
        <div class="icon">
            <figure>
                <img :src="data.icon" alt="" />
            </figure>
        </div>

        <div>
            <h2 class="title-city">{{ data.name }}</h2>
            <p class="temp">{{ data.temp }}º</p>
        </div>
    </article>
</template>

<script>
export default {
    props: {
        data: Object,
    },

    filters: {
        lower: function (value) {
            return value.toLowerCase();
        },
    },
};
</script>

<style>
article {
    width: 345px;
    height: 106px;
    background: #ffffff;
    box-shadow: 0px 4px 10px rgba(29, 54, 90, 0.08);
    border-radius: 10px;
    display: flex;
    align-items: center;
    color: #1d365a;
}

article .icon {
    width: 86px;
    height: 106px;

    border-radius: 10px 0px 0px 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-right: 15px;
}

article .title-city {
    font-size: 16px;
    font-weight: bold;
}

article .temp {
    font-weight: 300;
    font-size: 48px;
}

article.clouds .icon {
    background: linear-gradient(180deg, #1b76ff 0%, #bdd7ff 100%);
}

article.clear .icon {
    background: linear-gradient(180deg, #ff7d85 0%, #ff7e36 100%);
}
</style>