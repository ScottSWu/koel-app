<template>
    <article v-if="artist.id" id="artistInfo">
        <h1>
            <span>{{ artist.name }}</span>

            <a class="shuffle" @click.prevent="shuffleAll"><i class="fa fa-random"></i></a>
        </h1>

        <div v-if="artist.info">
            <img v-if="artist.info.image" :src="artist.info.image"
                title="They see me posin, they hatin"
                class="cool-guys-posing cover">

            <div class="bio" v-if="artist.info.bio.summary">
                <div class="summary" v-show="!showingFullBio">{{{ artist.info.bio.summary }}}</div>
                <div class="full" v-show="showingFullBio">{{{ artist.info.bio.full }}}</div>

                <button class="more" v-show="!showingFullBio" @click.prevent="showingFullBio = !showingFullBio">
                    Full Bio
                </button>
            </div>
            <p class="none" v-else>This artist has no Last.fm biography – yet.</p>

            <footer>Data &copy; <a target="_blank" href="{{{ artist.info.url }}}">Last.fm</a></footer>
        </div>

        <p class="none" v-else>Nothing can be found. This artist is a mystery.</p>
    </article>
</template>

<script>
    import playback from '../../../services/playback';

    export default {
        replace: false,
        props: ['artist'],

        data() {
            return {
                showingFullBio: false,
            };
        },

        methods: {
            /**
             * Reset the component's current state.
             */
            resetState() {
                this.showingFullBio = false;
            },

            /**
             * Shuffle all songs performed by the current song's artist.
             */
            shuffleAll() {
                playback.playAllByArtist(this.artist);
            },
        },
    };
</script>

<style lang="sass">
    @import "../../../sass/partials/_vars.scss";
    @import "../../../sass/partials/_mixins.scss";

    #artistInfo {
        img.cool-guys-posing {
            width: 100%;
            height: auto;
        }

        .bio {
            margin-top: 16px;
        }
    }
</style>
