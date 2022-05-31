<template>
<h3 class="bg-dark text-light">Music App</h3>
<div class="music">
    <section class="player">
        <h2 class="song-title">{{current.title}} - {{current.artist}}</h2>
        <div class="controls">
            <button @click="previous" class="btn btn-success  px-4 m-2">Previous</button>
            <button v-if="! isPlaying" @click="play" class="btn btn-danger px-5 m-2"> Play </button>
            <button v-if="isPlaying" @click="pause" class="btn btn-danger  px-5 m-2">Pause</button>
            <button @click="next" class="btn btn-success  px-5 m-2">Next</button>
        </div>

    </section>
    <section class="playlist">
        <h3>Your Playlist</h3>
        <ul v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src) ? 'text-danger':'text-secondary'">
            <li class="fs-5"> <span class="px-1">{{song.number}}</span><span class="px-3 fs-4">{{song.title}}</span>{{song.artist}}</li>
        </ul>

        <!--:class="(song.src == current.src) ? '':''-->

    </section>
</div>
</template>

<script>
export default {
    name: 'App',
    data() {
        return {
            isPlaying: false,
            current: [],
            index: 0,

            songs: [{
                    title: ' On My way',
                    artist: 'Alan Walker',
                    src: require('./assets/alan_walker_sabrina_carpenter_amp_farruko_on_my_way_mp3_50164.mp3'),
                    number: '1',
                },
                {
                    title: ' One Last time',
                    artist: 'Ariana Grande',
                    src: require('./assets/Ariana Grande - One Last Time (Lyric Video).mp3'),
                    number: '2',
                },
                {
                    title: ' Right Here',
                    artist: 'Brandy',
                    src: require('./assets/brandy_right_here.mp3'),
                    number: '3',
                },
                {
                    title: ' Shape Of You',
                    artist: 'Ed Sheeran',
                    src: require('./assets/ed_sheeran_shape_of_you_official_video_mp3_63995.mp3'),
                    number: '4',
                },
                {
                    title: ' Utawezana',
                    artist: 'Femi One',
                    src: require('./assets/femi_one_x_mejja_utawezana_official_video_mp3_61678.mp3'),
                    number: '5',
                },
                {
                    title: ' One More Night',
                    artist: 'Maroon 5',
                    src: require('./assets/maroon_5_one_more_night_mp3_64336.mp3'),
                    number: '6',
                },
                {
                    title: 'Steal My Girl ',
                    artist: 'One Direction',
                    src: require('./assets/one_direction_steal_my_girl_mp3_61785.mp3'),
                    number: '7',
                },
                {
                    title: ' Stay With Me',
                    artist: 'Romain Virgo',
                    src: require('./assets/Romain Virgo - Stay With Me (Reggae Cover) (1).mp3'),
                    number: '8',

                },
                {
                    title: ' Back To You',
                    artist: 'Selena Gomez',
                    src: require('./assets/selena_gomez_back_to_you_mp3_65021.mp3'),
                    number: '9',
                },
                {
                    title: ' The Script',
                    artist: 'Hall Of Fame',
                    src: require('./assets/The Script - Hall of Fame (Official Video) ft. will.i.am - YouTube (1).mp3'),
                    number: '10',
                },
                {
                    title: ' Stay',
                    artist: 'Zedd Alessia Cara',
                    src: require('./assets/Zedd_ Alessia Cara - Stay (Official Music Video).mp3'),
                    number: '11',
                }
            ],
            player: new Audio()
        }

    },
    created() {
        this.current = this.songs[this.index];
        this.player.src = this.current.src;

    },
    methods: {
        play(song) {
            if (typeof song.src != "undefined") {
                this.current = song;
                this.player.src = this.current.src;
            }

            this.player.play();
            this.isPlaying = true;

        },
        pause() {
            this.player.pause();
            this.isPlaying = false;

        },
        previous() {
            this.index--;
            if (this.index < 0) {
                this.index = this.songs.length - 1;

            }
            this.current = this.songs[this.index];
            this.play(this.current)
        },

        next() {
            this.index++;
            if (this.index > this.songs.length - 1) {
                this.index = 0;

            }
            this.current = this.songs[this.index];
            this.play(this.current)
        }
    }
}
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}

ul li {
    list-style-type: none;
}

.music {
    background: linear-gradient(45deg, darkgray, lightblue, lightgray, white, skyblue);
    background-size: 400% 400%;
    animation: one 10s ease-in-out infinite;
}

@keyframes one {
    0% {
        background-position: 0% 50%;
    }

    50% {
        background-position: 100% 50%;
    }

    100% {
        background-position: 0% 50%;
    }
}
</style>
